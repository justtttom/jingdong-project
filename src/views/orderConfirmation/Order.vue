<template>
    <div class="order">
        <div class="order__price">实付金额: <b>￥{{ calculations.price }}</b> </div>
        <div class="order__btn" @click="() => handleShowConfirmChange(true)">提交订单</div>
    </div>
    <div class="mask" v-show="showConfirm" @click="() => handleShowConfirmChange(false)">
        <div class="mask__content" @click.stop>
            <h3 class="mask__content__tittle">确认离开收银台？</h3>
            <p class="mask__content__desc">请尽快完成支付，否则将被取消！</p>
            <div class="mask__content__btns">
                <div class="mask__content__btn mask__content__btn--first" @click="() => handleConfirmOrder(true)">取消订单
                </div>
                <div class="mask__content__btn mask__content__btn--last" @click="() => handleConfirmOrder(false)">确认支付
                </div>
            </div>
        </div>
    </div>
    <Toast v-if="show" :message="toastMessage" />
</template>

<script>
import { ref } from 'vue'
import { useRouter, useRoute } from 'vue-router'
import { useStore } from 'vuex'
import { post } from '../../utils/request'
import { useCommonCartEffect } from '../../effects/cartEffects'
import Toast, { useToastEffect } from '../../components/Toast'

// 下单相关
const useMakeOrderEffect = () => {
    const route = useRoute()
    const router = useRouter()
    const store = useStore()
    const shopId = parseInt(route.params.id, 10)
    const { calculations, shopName, productList } = useCommonCartEffect(shopId)
    const { show, toastMessage, showToast } = useToastEffect()
    const handleConfirmOrder = async (isCanceled) => {
        const products = []
        for (let i in productList.value) {
            const product = productList.value[i]
            products.push({
                id: parseInt(product._id),
                num: product.count
            })
        }
        try {
            const result = await post('/api/order', {
                addressId: 1,
                shopId,
                shopName: shopName.vale,
                isCanceled,
                products,
            })
            if (result?.errno === 0) {
                store.commit('clearCartData', shopId)
                router.push({ name: 'OrderList' })
            } else {
                showToast('下单失败')
            }
        } catch (e) {
            showToast('请求失败')
        }
    }
    return { show, toastMessage, calculations, handleConfirmOrder }
}

// 蒙层提示
const useShowMaskEffect = () => {
    const showConfirm = ref(false)
    const handleShowConfirmChange = (status) => {
        showConfirm.value = status
    }
    return {showConfirm,handleShowConfirmChange}
}

export default {
    name: 'Order',
    components: { Toast },
    setup() {
        const { show, toastMessage, calculations, handleConfirmOrder } = useMakeOrderEffect()
        const {showConfirm,handleShowConfirmChange} = useShowMaskEffect()

        return { calculations, show, toastMessage, showConfirm, handleConfirmOrder, handleShowConfirmChange }
    }
}
</script>

<style lang="scss" scoped>
@import '../../style/viriables.scss';

.order {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    height: 0.49rem;
    line-height: .49rem;
    background: #FFF;

    &__price {
        flex: 1;
        font-size: .14rem;
        text-indent: .24rem;
        color: $content-fontColor;

    }

    &__btn {
        width: 0.98rem;
        text-align: center;
        color: #FFF;
        font-size: .14rem;
        background: $btn-bgColor ;
    }
}

.mask {
    z-index: 1;
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    top: 0;
    background: rgba(0, 0, 0, 0.50);

    &__content {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 3rem;
        height: 1.50rem;
        background: #FFFFFF;
        border-radius: .04rem;
        text-align: center;

        &__tittle {
            margin: .24rem 0 0 0;
            line-height: .26rem;
            font-size: .18rem;
            color: $content-fontColor;
        }

        &__desc {
            margin: .08rem 0 0 0;
            line-height: .2rem;
            font-size: .14rem;
            color: #666666;
        }

        &__btns {
            display: flex;
            margin: .24rem .58rem;
        }

        &__btn {
            flex: 1;
            width: 0.8rem;
            line-height: .32rem;
            border: .01rem solid #4FB0F9;
            border-radius: .16rem;

            &--first {
                margin-right: .12rem;
                font-size: .14rem;
                color: $btn-bgColor;
            }

            &--last {
                margin-left: .12rem;
                font-size: .14rem;
                background: #4FB0F9;
                color: $bgColor;
            }
        }
    }
}
</style>